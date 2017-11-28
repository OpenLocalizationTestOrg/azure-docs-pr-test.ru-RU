---
title: "вход в приложение tooan из панели доступа hello aaaProblems | Документы Microsoft"
description: "Как tootroubleshoot проблемы с доступом к приложению из hello панели доступа Microsoft Azure AD на сайте myapps.microsoft.com"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="b140d-103">Проблемы со входом в приложение tooan из панели доступа hello</span><span class="sxs-lookup"><span data-stu-id="b140d-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="b140d-104">Hello панель доступа является Интернет-порталом, который позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, hello администратор Azure AD им предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="b140d-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="b140d-105">Эти приложения настроены от имени пользователя hello hello портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="b140d-106">Hello приложения должны быть правильно настроены и назначенный toohello пользователя или пользователя hello группы входит toosee приложения hello в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b140d-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="b140d-107">Тип приложения, которые пользователь может видеть Hello, попадают в hello следующие категории:</span><span class="sxs-lookup"><span data-stu-id="b140d-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="b140d-108">приложения Office 365;</span><span class="sxs-lookup"><span data-stu-id="b140d-108">Office 365 Applications</span></span>

-   <span data-ttu-id="b140d-109">приложения Майкрософт и сторонние приложения с единым входом на основе федерации;</span><span class="sxs-lookup"><span data-stu-id="b140d-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="b140d-110">приложения с единым входом на основе паролей;</span><span class="sxs-lookup"><span data-stu-id="b140d-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="b140d-111">приложения с существующими решениями единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="b140d-112">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="b140d-112">General issues toocheck first</span></span>

-   <span data-ttu-id="b140d-113">Убедитесь, что с вашей помощью **браузера** , удовлетворяющей hello минимальным требованиям для hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b140d-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="b140d-114">Убедитесь, что браузер пользователя hello добавил hello URL-адрес tooits приложения hello **надежные сайты**.</span><span class="sxs-lookup"><span data-stu-id="b140d-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="b140d-115">Убедитесь, что приложение hello toocheck **настроен** правильно.</span><span class="sxs-lookup"><span data-stu-id="b140d-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="b140d-116">Убедитесь, что учетная запись пользователя hello **включен** для входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="b140d-117">Убедитесь, что учетная запись пользователя hello **не заблокирована.**</span><span class="sxs-lookup"><span data-stu-id="b140d-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="b140d-118">Убедитесь, что пользователь hello **не просрочен или забудете пароль.**</span><span class="sxs-lookup"><span data-stu-id="b140d-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="b140d-119">Проверьте, не блокирует ли **Многофакторная Идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="b140d-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="b140d-120">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="b140d-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="b140d-121">Убедитесь, что пользователь **контактные сведения для проверки подлинности** работает toodate tooallow многофакторной проверки подлинности или условного доступа политики toobe принудительно.</span><span class="sxs-lookup"><span data-stu-id="b140d-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="b140d-122">Убедитесь, что tooalso try очистки файлов cookie в браузере и повторить попытку toosign в.</span><span class="sxs-lookup"><span data-stu-id="b140d-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="b140d-123">Соответствующие требования к браузеру для hello панели доступа</span><span class="sxs-lookup"><span data-stu-id="b140d-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="b140d-124">Hello панели доступа требуется браузер, поддерживающий JavaScript и CSS включена.</span><span class="sxs-lookup"><span data-stu-id="b140d-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="b140d-125">toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="b140d-126">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="b140d-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="b140d-127">Для единого входа по паролю может быть браузеров hello конечных пользователей:</span><span class="sxs-lookup"><span data-stu-id="b140d-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="b140d-128">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="b140d-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="b140d-129">Edge в Windows 10 Anniversary Edition или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="b140d-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="b140d-130">Chrome (начиная с Windows 7 и Mac OS X);</span><span class="sxs-lookup"><span data-stu-id="b140d-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="b140d-131">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="b140d-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="b140d-132">Как tooinstall hello расширение обозревателя панели доступа</span><span class="sxs-lookup"><span data-stu-id="b140d-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="b140d-133">hello tooinstall расширение обозревателя панели доступа, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-134">Откройте hello [панели доступа](https://myapps.microsoft.com) в одном hello поддерживаемых браузеров и входа в качестве **пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b140d-135">Нажмите кнопку **SSO на ОСНОВЕ пароля приложения** в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b140d-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="b140d-136">В hello запрос запросом tooinstall hello программного обеспечения, выберите **установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="b140d-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b140d-137">На основе браузера можно направленной toohello ссылку для скачивания.</span><span class="sxs-lookup"><span data-stu-id="b140d-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="b140d-138">**Добавить** браузер tooyour расширений hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="b140d-139">Если браузер запрашивает, выберите tooeither **включить** или **Разрешить** hello расширения.</span><span class="sxs-lookup"><span data-stu-id="b140d-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="b140d-140">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="b140d-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b140d-141">Войдите в панель доступа hello и разделе, если вы можете **запуска** приложения SSO на ОСНОВЕ пароля</span><span class="sxs-lookup"><span data-stu-id="b140d-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b140d-142">Можно также загрузить расширения hello для Chrome и границей из hello прямые ссылки ниже:</span><span class="sxs-lookup"><span data-stu-id="b140d-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="b140d-143">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="b140d-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b140d-144">Расширение "Панель доступа" для Edge</span><span class="sxs-lookup"><span data-stu-id="b140d-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b140d-145">Как tooconfigure федеративного единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="b140d-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="b140d-146">Все приложения в коллекции Azure AD hello включен с возможностью корпоративного единого входа имеет доступные Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="b140d-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="b140d-147">Можно получить доступ к hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) Подробное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="b140d-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="b140d-148">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="b140d-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b140d-149">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="b140d-150">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="b140d-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b140d-151">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="b140d-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b140d-152">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="b140d-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b140d-153">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="b140d-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b140d-154">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="b140d-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b140d-155">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b140d-156">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-157">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="b140d-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b140d-158">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-159">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-160">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-161">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="b140d-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b140d-162">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="b140d-163">Выберите приложение hello, требуется tooconfigure для единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="b140d-164">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b140d-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b140d-165">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b140d-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b140d-166">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b140d-167">Настройка единого входа для приложения из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b140d-168">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-170">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-171">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-172">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-173">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b140d-174">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-175">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b140d-176">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-177">Выберите **входа на базе SAML** из hello **режим** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b140d-178">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="b140d-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b140d-179">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="b140d-180">приложение hello tooconfigure как единый вход, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b140d-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="b140d-181">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b140d-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="b140d-182">приложение hello tooconfigure как инициированный IdP SSO, hello URL-адрес ответа является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b140d-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="b140d-183">Для некоторых приложений hello идентификатор также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b140d-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="b140d-184">**Необязательно:** щелкните **Показывать дополнительные параметры URL-адреса** Если требуется toosee hello необязательные значения.</span><span class="sxs-lookup"><span data-stu-id="b140d-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="b140d-185">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="b140d-186">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b140d-187">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="b140d-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b140d-188">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="b140d-188">click **Add attribute**.</span></span> <span data-ttu-id="b140d-189">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b140d-190">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b140d-190">Click **Save.**</span></span> <span data-ttu-id="b140d-191">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="b140d-192">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b140d-193">Кроме того имеет URL-адреса метаданных hello и toosetup требуется сертификат для единого входа с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="b140d-194">Нажмите кнопку **Сохранить** toosave hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b140d-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="b140d-195">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b140d-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b140d-196">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="b140d-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b140d-197">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-198">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-199">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-200">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-201">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-202">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b140d-203">Если hello приложение, tooshow здесь не отображается, используйте hello **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-204">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b140d-205">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-206">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b140d-207">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b140d-208">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="b140d-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b140d-209">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="b140d-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="b140d-210">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b140d-211">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="b140d-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b140d-212">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="b140d-212">click **Add attribute**.</span></span> <span data-ttu-id="b140d-213">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b140d-214">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b140d-214">Click **Save.**</span></span> <span data-ttu-id="b140d-215">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b140d-216">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="b140d-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b140d-217">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-218">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-219">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-220">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-221">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-222">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b140d-223">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-224">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b140d-225">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-226">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="b140d-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b140d-227">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="b140d-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="b140d-228">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b140d-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b140d-229">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="b140d-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b140d-230">Как tooconfigure федеративного единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="b140d-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b140d-231">tooconfigure приложения не коллекции требуется toohave Azure AD premium и SAML 2.0 поддерживает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="b140d-232">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b140d-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="b140d-233">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="b140d-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="b140d-234">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="b140d-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b140d-235">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="b140d-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b140d-236">Настройка значения метаданных Azure AD в приложение hello (вход, URL-адрес, издателя, URL-адрес выхода и сертификата)</span><span class="sxs-lookup"><span data-stu-id="b140d-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="b140d-237">Настройка значения метаданных приложения hello в Azure AD (вход, URL-адрес ответа URL-адрес, идентификатор)</span><span class="sxs-lookup"><span data-stu-id="b140d-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="b140d-238">tooconfigure единого входа для приложения, которое не находится в коллекции hello Azure AD, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-239">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-240">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-241">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-242">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-243">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="b140d-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b140d-244">Нажмите кнопку **приложения коллекции не** в hello **добавить собственное приложение** раздела</span><span class="sxs-lookup"><span data-stu-id="b140d-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="b140d-245">Введите имя приложения hello hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b140d-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="b140d-246">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b140d-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="b140d-247">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="b140d-248">Выберите **входа на базе SAML** в hello **режим** раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="b140d-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="b140d-249">Введите значения требуется hello в **URL-адреса и домена.**</span><span class="sxs-lookup"><span data-stu-id="b140d-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b140d-250">Вы должны получить эти значения с поставщиком приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="b140d-251">приложение hello tooconfigure как единый вход, инициированный IdP, введите URL-адрес ответа hello и hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b140d-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="b140d-252">**Необязательно:** tooconfigure приложения hello в виде единого входа, инициированные SP, hello входа на URL-адрес является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b140d-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="b140d-253">В hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="b140d-254">**Необязательно:** щелкните **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b140d-255">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="b140d-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="b140d-256">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="b140d-256">click **Add attribute**.</span></span> <span data-ttu-id="b140d-257">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b140d-258">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b140d-258">Click **Save.**</span></span> <span data-ttu-id="b140d-259">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="b140d-260">Нажмите кнопку **Настройка &lt;имя_приложения&gt;**  tooaccess документацию по tooconfigure единого входа в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b140d-261">Кроме того имеет URL-адреса Azure AD и сертификат, необходимый для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b140d-262">Выберите идентификатор пользователя и добавить приложение toohello toobe отправлено атрибуты пользователя</span><span class="sxs-lookup"><span data-stu-id="b140d-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b140d-263">tooselect hello идентификатор пользователя или добавление атрибутов пользователя, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-264">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-265">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-266">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-267">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-268">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b140d-269">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-270">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b140d-271">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-272">В разделе hello **атрибуты пользователя** выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b140d-273">Hello выбранного параметра должен toomatch hello ожидаемое значение в tooauthenticate hello hello приложения пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b140d-274">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="b140d-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b140d-275">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="b140d-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="b140d-276">атрибуты пользователя tooadd, нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** tooedit hello атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="b140d-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b140d-277">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="b140d-277">tooadd an attribute:</span></span>

   <span data-ttu-id="b140d-278">1. Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="b140d-278">1.click **Add attribute**.</span></span> <span data-ttu-id="b140d-279">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="b140d-280">2. Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b140d-280">2 Click **Save.**</span></span> <span data-ttu-id="b140d-281">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b140d-282">Загрузка метаданных Azure AD hello или сертификат</span><span class="sxs-lookup"><span data-stu-id="b140d-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b140d-283">метаданные приложения hello toodownload или сертификат от Azure AD, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-284">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-285">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-286">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-287">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-288">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b140d-289">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-290">Выберите приложение hello настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b140d-291">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-292">Go слишком**сертификат подписи SAML** статьи, а затем нажмите кнопку **загрузки** значение столбца.</span><span class="sxs-lookup"><span data-stu-id="b140d-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b140d-293">В зависимости от того, какое приложение hello требуется настроить единый вход вы увидите либо параметр toodownload hello hello метаданные в формате XML или hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="b140d-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="b140d-294">Azure AD не предоставляет метаданных hello tooget URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b140d-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b140d-295">Hello метаданные могут быть получены только как XML-файл.</span><span class="sxs-lookup"><span data-stu-id="b140d-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b140d-296">Как tooconfigure пароля единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="b140d-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="b140d-297">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="b140d-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b140d-298">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="b140d-299">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b140d-300">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b140d-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b140d-301">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-302">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="b140d-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b140d-303">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-304">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-305">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-306">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="b140d-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b140d-307">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello</span><span class="sxs-lookup"><span data-stu-id="b140d-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="b140d-308">Выберите hello приложение tooconfigure для единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="b140d-309">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b140d-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b140d-310">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b140d-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b140d-311">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="b140d-312">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="b140d-313">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-314">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-315">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-316">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-317">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-318">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="b140d-319">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-320">Выберите hello приложение tooconfigure единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="b140d-321">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-322">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="b140d-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b140d-323">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b140d-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="b140d-324">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="b140d-325">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="b140d-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b140d-326">Как tooconfigure пароля единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="b140d-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b140d-327">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="b140d-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="b140d-328">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="b140d-328">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="b140d-329">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="b140d-330">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="b140d-330">Add a non-gallery application</span></span>

<span data-ttu-id="b140d-331">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-332">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="b140d-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b140d-333">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-334">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-335">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-336">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="b140d-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b140d-337">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="b140d-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="b140d-338">Введите имя приложения hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b140d-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="b140d-339">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b140d-339">Select **Add.**</span></span>

<span data-ttu-id="b140d-340">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="b140d-341">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="b140d-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="b140d-342">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-343">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="b140d-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b140d-344">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-345">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-346">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-347">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="b140d-348">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-349">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="b140d-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b140d-350">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-351">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="b140d-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b140d-352">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="b140d-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="b140d-353">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="b140d-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="b140d-354">Убедитесь, что вход hello поля отображаются по URL-АДРЕСУ hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="b140d-355">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b140d-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="b140d-356">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="b140d-357">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="b140d-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="b140d-358">Как tooassign пользовательским tooan приложением напрямую</span><span class="sxs-lookup"><span data-stu-id="b140d-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="b140d-359">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b140d-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="b140d-360">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="b140d-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b140d-361">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="b140d-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b140d-362">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="b140d-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b140d-363">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b140d-364">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="b140d-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b140d-365">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="b140d-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b140d-366">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="b140d-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="b140d-367">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b140d-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b140d-368">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="b140d-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b140d-369">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="b140d-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b140d-370">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b140d-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b140d-371">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="b140d-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="b140d-372">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="b140d-373">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="b140d-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="b140d-374">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="b140d-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="b140d-375">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="b140d-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="b140d-376">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b140d-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="b140d-377">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b140d-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="b140d-378">Если эти действия по устранению неполадок не hello устраните проблему hello</span><span class="sxs-lookup"><span data-stu-id="b140d-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="b140d-379">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="b140d-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="b140d-380">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="b140d-380">Correlation error ID</span></span>

-   <span data-ttu-id="b140d-381">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="b140d-381">UPN (user email address)</span></span>

-   <span data-ttu-id="b140d-382">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="b140d-382">TenantID</span></span>

-   <span data-ttu-id="b140d-383">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="b140d-383">Browser type</span></span>

-   <span data-ttu-id="b140d-384">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="b140d-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b140d-385">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b140d-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b140d-386">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b140d-386">Next steps</span></span>
[<span data-ttu-id="b140d-387">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="b140d-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

