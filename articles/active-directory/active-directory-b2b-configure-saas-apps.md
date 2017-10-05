---
title: "Настройка приложений SaaS для службы совместной работы B2B в Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="ec661-103">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="ec661-104">Служба совместной работы Azure Active Directory (Azure AD) B2B работает с большинством приложений, которые интегрируются с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec661-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="ec661-105">Этот раздел содержит пошаговые инструкции по настройке некоторых популярных приложений SAS для использования со службой Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="ec661-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="ec661-106">Прежде чем рассматривать инструкции для конкретного приложения, ознакомьтесь с общими правилами.</span><span class="sxs-lookup"><span data-stu-id="ec661-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="ec661-107">В большинстве приложений пользователя следует настраивать вручную.</span><span class="sxs-lookup"><span data-stu-id="ec661-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="ec661-108">Это значит, что создавать пользователя тоже нужно вручную в приложении.</span><span class="sxs-lookup"><span data-stu-id="ec661-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="ec661-109">В приложениях, поддерживающих автоматическую настройку, например в Dropbox, создаются отдельные приглашения.</span><span class="sxs-lookup"><span data-stu-id="ec661-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="ec661-110">Пользователи должны принять каждое приглашение.</span><span class="sxs-lookup"><span data-stu-id="ec661-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="ec661-111">Чтобы избежать проблем с искажением диска профиля пользователя (UPD) в гостевых пользователях, в атрибутах пользователя всегда выбирайте **user.mail** в качестве **идентификатора пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ec661-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="ec661-112">Dropbox для бизнеса</span><span class="sxs-lookup"><span data-stu-id="ec661-112">Dropbox Business</span></span>

<span data-ttu-id="ec661-113">Чтобы пользователи могли войти, используя свою учетную запись организации, необходимо вручную настроить Dropbox для бизнеса для использования Azure AD в качестве поставщика удостоверений языка разметки заявлений системы безопасности (SAML).</span><span class="sxs-lookup"><span data-stu-id="ec661-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="ec661-114">Если не настроить Dropbox для бизнеса таким образом, приложение не будет запрашивать ввод учетных данных или другим способом позволять пользователям входить с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec661-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="ec661-115">Чтобы добавить приложение Dropbox для бизнеса в Azure AD, выберите на панели слева раздел **Корпоративные приложения**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec661-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Кнопка "Добавить" в разделе "Корпоративные приложения"](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="ec661-117">В окне **Добавить приложение** введите **dropbox** в поле поиска, а затем выберите в списке результатов **Dropbox для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="ec661-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Поиск dropbox на странице добавления приложения](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="ec661-119">На странице **Единый вход** выберите на панели слева **Единый вход**, а затем введите **user.mail** в поле **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ec661-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="ec661-120">(Этот идентификатор задан как имя участника-пользователя по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ec661-120">(It's set as UPN by default.)</span></span>

  ![Настройка единого входа для приложения](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="ec661-122">Чтобы загрузить сертификат для использования при настройке Dropbox, выберите **Настройка Dropbox**, а затем выберите в списке **URL-адрес службы единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="ec661-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Скачивание сертификата, который будет использоваться для настройки Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="ec661-124">Войдите в Dropbox с помощью URL-адреса входа со страницы **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ec661-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Страница входа в Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="ec661-126">Выберите в меню **Консоль администратора**.</span><span class="sxs-lookup"><span data-stu-id="ec661-126">On the menu, select **Admin Console**.</span></span>

  ![Ссылка "Консоль администратора" в меню Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="ec661-128">В диалоговом окне **Проверка подлинности** выберите **Подробнее**, передайте сертификат, а затем в поле **URL-адрес входа** введите URL-адрес единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="ec661-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Ссылка "Подробнее" в свернутом диалоговом окне проверки подлинности](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![URL-адрес входа в развернутом диалоговом окне проверки подлинности](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="ec661-131">Чтобы настроить автоматическую подготовку пользователя на портале Azure, щелкните на левой панели раздел **Подготовка**, выберите значение **Автоматически** в поле **Режим подготовки**, а затем нажмите кнопку **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="ec661-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Настройка автоматической подготовки пользователей на портале Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="ec661-133">После подготовки гостя или участника в приложении Dropbox эти пользователи получают отдельные приглашения из Dropbox.</span><span class="sxs-lookup"><span data-stu-id="ec661-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="ec661-134">Чтобы использовать единый вход Dropbox, приглашенные пользователи должны принять приглашение, щелкнув ссылку в нем.</span><span class="sxs-lookup"><span data-stu-id="ec661-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="ec661-135">Box</span><span class="sxs-lookup"><span data-stu-id="ec661-135">Box</span></span>
<span data-ttu-id="ec661-136">Вы можете разрешить пользователям проверять подлинность гостевых пользователей Box с помощью учетной записью Azure AD, используя федерацию, основанную на протоколе SAML.</span><span class="sxs-lookup"><span data-stu-id="ec661-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="ec661-137">Для этого нужно отправить метаданные на сайт Box.com.</span><span class="sxs-lookup"><span data-stu-id="ec661-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="ec661-138">Добавьте приложение Box из корпоративных приложений.</span><span class="sxs-lookup"><span data-stu-id="ec661-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="ec661-139">Настройте единый вход, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ec661-139">Configure single sign-on in the following order:</span></span>

  ![Настройте единый вход в Box.](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="ec661-141">а.</span><span class="sxs-lookup"><span data-stu-id="ec661-141">a.</span></span> <span data-ttu-id="ec661-142">Проверьте поле **URL-адрес для входа**, чтобы убедиться, что на портале Azure указан правильный URL-адрес для Box.</span><span class="sxs-lookup"><span data-stu-id="ec661-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="ec661-143">Этот URL-адрес совпадает с URL-адресом вашего клиента Box.com.</span><span class="sxs-lookup"><span data-stu-id="ec661-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="ec661-144">Он должен соответствовать условиям соглашения об именовании *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="ec661-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="ec661-145">**Идентификатор** не применяется к этому приложению, но это поле по-прежнему отображается как обязательное.</span><span class="sxs-lookup"><span data-stu-id="ec661-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="ec661-146">b.</span><span class="sxs-lookup"><span data-stu-id="ec661-146">b.</span></span> <span data-ttu-id="ec661-147">В поле **Идентификатор пользователя** введите **user.mail** (для единого входа для учетных записей гостей).</span><span class="sxs-lookup"><span data-stu-id="ec661-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="ec661-148">c.</span><span class="sxs-lookup"><span data-stu-id="ec661-148">c.</span></span> <span data-ttu-id="ec661-149">В разделе **Сертификат подписи SAML** щелкните **Создать сертификат**.</span><span class="sxs-lookup"><span data-stu-id="ec661-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="ec661-150">г)</span><span class="sxs-lookup"><span data-stu-id="ec661-150">d.</span></span> <span data-ttu-id="ec661-151">Чтобы настроить клиент Box.com для использования в качестве поставщика удостоверений Azure AD, скачайте файл метаданных и сохраните его на локальный диск.</span><span class="sxs-lookup"><span data-stu-id="ec661-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="ec661-152">д.</span><span class="sxs-lookup"><span data-stu-id="ec661-152">e.</span></span> <span data-ttu-id="ec661-153">Перешлите файл метаданных группе поддержки Box, которая настраивает для вас единый вход.</span><span class="sxs-lookup"><span data-stu-id="ec661-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="ec661-154">Чтобы настроить автоматическую подготовку пользователей в Azure AD, на левой панели выберите **Подготовка**, а затем нажмите кнопку **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="ec661-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Авторизация Azure AD для подключения к Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="ec661-156">Как и в Dropbox, приглашенные Box также должны активировать свои приглашения.</span><span class="sxs-lookup"><span data-stu-id="ec661-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec661-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec661-157">Next steps</span></span>

<span data-ttu-id="ec661-158">Другие статьи о службе совместной работы Azure AD B2B перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="ec661-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ec661-159">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="ec661-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ec661-160">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="ec661-161">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="ec661-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ec661-162">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ec661-163">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="ec661-164">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ec661-165">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ec661-166">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec661-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ec661-167">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="ec661-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ec661-168">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="ec661-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
