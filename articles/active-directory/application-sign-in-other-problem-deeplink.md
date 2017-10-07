---
title: "вход в приложение tooan, с помощью прямой ссылки aaaProblems | Документы Microsoft"
description: "Как tootroubleshoot проблемы с доступом к приложению из URL-адрес прямой ссылки, с помощью Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="2df7c-103">Проблемы со входом в приложение tooan, с помощью прямой ссылки</span><span class="sxs-lookup"><span data-stu-id="2df7c-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="2df7c-104">Hello панель доступа является Интернет-порталом, который позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, hello администратор Azure AD им предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="2df7c-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="2df7c-105">Эти приложения настроены от имени пользователя hello hello портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2df7c-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="2df7c-106">Hello приложения должны быть правильно настроены и назначенный toohello пользователя или пользователя hello группы входит toosee приложения hello в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="2df7c-107">Прямые ссылки или пользователя URL-адреса являются ссылками, пользователи могут использовать tooaccess свои приложения SSO на ОСНОВЕ пароля непосредственно из URL-адреса своих браузерах панелей.</span><span class="sxs-lookup"><span data-stu-id="2df7c-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="2df7c-108">Изучив toothis ссылку, пользователи автоматически быть вход в приложение hello без необходимости сначала toogo toohello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="2df7c-109">Это hello же ссылку, чтобы пользователи использовали tooaccess эти приложения с запуска приложения hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="2df7c-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="2df7c-110">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="2df7c-110">General issues toocheck first</span></span>

-   <span data-ttu-id="2df7c-111">Убедитесь, что с вашей помощью **браузера** , удовлетворяющей hello минимальным требованиям для hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="2df7c-112">Убедитесь, что браузер пользователя hello добавил hello URL-адрес tooits приложения hello **надежные сайты**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="2df7c-113">Убедитесь, что приложение hello toocheck **настроен** правильно.</span><span class="sxs-lookup"><span data-stu-id="2df7c-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="2df7c-114">Убедитесь, что учетная запись пользователя hello **включен** для входа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="2df7c-115">Убедитесь, что учетная запись пользователя hello **не заблокирована.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="2df7c-116">Убедитесь, что пользователь hello **не просрочен или забудете пароль.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="2df7c-117">Проверьте, не блокирует ли **Многофакторная Идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="2df7c-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="2df7c-118">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="2df7c-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="2df7c-119">Убедитесь, что пользователь **контактные сведения для проверки подлинности** работает toodate tooallow многофакторной проверки подлинности или условного доступа политики toobe принудительно.</span><span class="sxs-lookup"><span data-stu-id="2df7c-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="2df7c-120">Убедитесь, что tooalso try очистки файлов cookie в браузере и повторить попытку toosign в.</span><span class="sxs-lookup"><span data-stu-id="2df7c-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="2df7c-121">Проверка прямой ссылки hello</span><span class="sxs-lookup"><span data-stu-id="2df7c-121">Checking hello deeplink</span></span>

<span data-ttu-id="2df7c-122">toocheck, если у вас есть правильный прямой ссылки hello, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="2df7c-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-123">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2df7c-124">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-125">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-126">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-127">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="2df7c-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2df7c-128">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2df7c-129">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="2df7c-130">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="2df7c-131">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="2df7c-132">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="2df7c-133">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="2df7c-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2df7c-134">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="2df7c-135">Выберите приложение hello hello проверка hello и прямой ссылки для.</span><span class="sxs-lookup"><span data-stu-id="2df7c-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="2df7c-136">Найти метку hello **URL-адрес пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="2df7c-137">Прямая ссылка должна соответствовать этому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="2df7c-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="2df7c-138">Как tooinstall hello расширение обозревателя панели доступа</span><span class="sxs-lookup"><span data-stu-id="2df7c-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="2df7c-139">hello tooinstall расширение обозревателя панели доступа, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="2df7c-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-140">Откройте hello [панели доступа](https://myapps.microsoft.com) в одном hello поддерживаемых браузеров и входа в качестве **пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2df7c-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="2df7c-141">Нажмите кнопку **SSO на ОСНОВЕ пароля приложения** в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="2df7c-142">В hello запрос запросом tooinstall hello программного обеспечения, выберите **установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="2df7c-143">На основе браузера можно направленной toohello ссылку для скачивания.</span><span class="sxs-lookup"><span data-stu-id="2df7c-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="2df7c-144">**Добавить** браузер tooyour расширений hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="2df7c-145">Если браузер запрашивает, выберите tooeither **включить** или **Разрешить** hello расширения.</span><span class="sxs-lookup"><span data-stu-id="2df7c-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="2df7c-146">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="2df7c-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="2df7c-147">Войдите в панель доступа hello и разделе, если вы можете **запуска** приложения SSO на ОСНОВЕ пароля</span><span class="sxs-lookup"><span data-stu-id="2df7c-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="2df7c-148">Можно также загрузить расширения hello Chrome и Firefox из hello прямые ссылки ниже:</span><span class="sxs-lookup"><span data-stu-id="2df7c-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="2df7c-149">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="2df7c-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="2df7c-150">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="2df7c-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="2df7c-151">Как tooconfigure пароля единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="2df7c-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="2df7c-152">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="2df7c-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2df7c-153">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2df7c-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="2df7c-154">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="2df7c-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="2df7c-155">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2df7c-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="2df7c-156">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-157">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="2df7c-158">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-159">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-160">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-161">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="2df7c-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2df7c-162">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="2df7c-163">Выберите приложение hello, требуется tooconfigure для единого входа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="2df7c-164">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="2df7c-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="2df7c-165">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2df7c-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="2df7c-166">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2df7c-167">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="2df7c-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2df7c-168">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-169">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2df7c-170">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-171">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-172">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-173">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="2df7c-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2df7c-174">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2df7c-175">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2df7c-176">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2df7c-177">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2df7c-178">[Назначить пользователей приложения toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="2df7c-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="2df7c-179">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2df7c-180">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="2df7c-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="2df7c-181">Как tooconfigure пароля единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="2df7c-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="2df7c-182">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="2df7c-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="2df7c-183">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="2df7c-183">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="2df7c-184">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="2df7c-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="2df7c-185">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="2df7c-185">Add a non-gallery application</span></span>

<span data-ttu-id="2df7c-186">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-187">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="2df7c-188">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-189">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-190">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-191">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку.</span><span class="sxs-lookup"><span data-stu-id="2df7c-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2df7c-192">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="2df7c-193">Введите имя приложения hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="2df7c-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="2df7c-194">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-194">Select **Add.**</span></span>

<span data-ttu-id="2df7c-195">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2df7c-196">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="2df7c-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2df7c-197">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-198">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2df7c-199">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-200">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-201">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-202">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="2df7c-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="2df7c-203">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2df7c-204">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2df7c-205">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2df7c-206">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2df7c-207">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="2df7c-208">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="2df7c-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="2df7c-209">Убедитесь, что вход hello поля отображаются по URL-АДРЕСУ hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="2df7c-210">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="2df7c-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="2df7c-211">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2df7c-212">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="2df7c-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="2df7c-213">Как tooassign пользовательским tooan приложением напрямую</span><span class="sxs-lookup"><span data-stu-id="2df7c-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="2df7c-214">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2df7c-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="2df7c-215">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2df7c-216">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="2df7c-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2df7c-217">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="2df7c-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2df7c-218">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2df7c-219">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="2df7c-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2df7c-220">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="2df7c-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2df7c-221">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="2df7c-222">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2df7c-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2df7c-223">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="2df7c-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2df7c-224">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="2df7c-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2df7c-225">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="2df7c-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2df7c-226">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="2df7c-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="2df7c-227">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="2df7c-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="2df7c-228">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="2df7c-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="2df7c-229">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="2df7c-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="2df7c-230">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="2df7c-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="2df7c-231">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2df7c-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="2df7c-232">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2df7c-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="2df7c-233">Если эти действия по устранению неполадок не hello устраните проблему hello.</span><span class="sxs-lookup"><span data-stu-id="2df7c-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="2df7c-234">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="2df7c-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="2df7c-235">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="2df7c-235">Correlation error ID</span></span>

-   <span data-ttu-id="2df7c-236">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="2df7c-236">UPN (user email address)</span></span>

-   <span data-ttu-id="2df7c-237">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="2df7c-237">TenantID</span></span>

-   <span data-ttu-id="2df7c-238">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="2df7c-238">Browser type</span></span>

-   <span data-ttu-id="2df7c-239">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="2df7c-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="2df7c-240">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="2df7c-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="2df7c-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2df7c-241">Next steps</span></span>
[<span data-ttu-id="2df7c-242">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="2df7c-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
